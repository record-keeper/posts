# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-10T12:40:04.260592+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×26 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×26 (24h)
- 🔴 CALIBRATION_DRIFT×23 (24h)
- 🟡 FINAL_MISSING×19 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-10T12:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CALIBRATION_DRIFT  ×38  [2026-09-10T12:02:32]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×46  [2026-09-10T12:02:32]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×45  [2026-09-10T12:02:32]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×38  [2026-09-10T12:02:32]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×44  [2026-09-10T11:16:26]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×28  [2026-09-10T10:37:49]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-10T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=84<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-10T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S00: n=182<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-09-10T06:00:16]
- key: `ORPHAN_SCAN|194 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-10T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=190<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-10T06:00:16]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1773 actual=0.2222 gap=-0.0449`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-10T06:00:16]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=46 pred=0.3225 actual=0.3043 gap=+0.0182`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-10T06:00:16]
- key: `ROI_STAT|S00: n=182 hit%=26.4% hit_CI[Bonf]=[18.1,36.7]% ROI=0.90 ROI_boot95=[0.64,1.19]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-10T06:00:16]
- key: `ROI_STAT|S01_NAKAANA1: n=190 hit%=23.7% hit_CI[Bonf]=[16.0,33.6]% ROI=0.74 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-10T06:00:16]
- key: `ROI_STAT|S02_TETSUBAN: n=84 hit%=35.7% hit_CI[Bonf]=[22.6,51.5]% ROI=0.63 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-10T06:00:16]
- key: `DRIFT_BUCKET|drift ≤-30%: n=38 hit%=21.1% ROI=0.63 (コスト 10,700/回収 6,700)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-10T06:00:16]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=43 hit%=30.2% ROI=0.96 (コスト 10,000/回収 9,640)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-10T06:00:16]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=99 hit%=26.3% ROI=0.92 (コスト 22,800/回収 20,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-10T06:00:16]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=44 hit%=18.2% ROI=0.32 (コスト 9,500/回収 3,080)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 12.81MB / last modified 2026-09-10T12:39:30.977123+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
00} default=5000
2026-09-10 12:39:05,736 [INFO] predictor: Models loaded OK
2026-09-10 12:39:17,116 [INFO] scraper: odds3t: 120/120 parsed
2026-09-10 12:39:18,288 [INFO] scraper: odds3f: 20/20 parsed
2026-09-10 12:39:19,379 [INFO] scraper: odds2t: 30/30 parsed
2026-09-10 12:39:19,380 [INFO] scraper: odds2f: 15/15 parsed
2026-09-10 12:39:20,480 [INFO] scraper: odds_win: 4/6 parsed
2026-09-10 12:39:20,480 [INFO] scraper: fetch_race 17/5: boats=6 odds=189/191
2026-09-10 12:39:20,484 [INFO] predictor: CALIBRATION_MODE=on
2026-09-10 12:39:20,484 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-09-10 12:39:20,488 [INFO] run_cycle: fetched 17/5 [final]: 154 combos
2026-09-10 12:39:24,149 [INFO] scraper: odds3t: 120/120 parsed
2026-09-10 12:39:25,247 [INFO] scraper: odds3f: 20/20 parsed
2026-09-10 12:39:26,382 [INFO] scraper: odds2t: 30/30 parsed
2026-09-10 12:39:26,384 [INFO] scraper: odds2f: 15/15 parsed
2026-09-10 12:39:27,454 [INFO] scraper: odds_win: 3/6 parsed
2026-09-10 12:39:27,454 [INFO] scraper: fetch_race 04/5: boats=6 odds=188/191
2026-09-10 12:39:27,456 [INFO] predictor: CALIBRATION_MODE=on
2026-09-10 12:39:27,457 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-09-10 12:39:27,460 [INFO] run_cycle: fetched 04/5 [scan]: 153 combos
2026-09-10 12:39:27,984 [INFO] race_id: notif: nid=2026091004051252 sid=S00 phase=scan rank=SS
2026-09-10 12:39:28,460 [INFO] notifier: Discord notify OK (status=204)
2026-09-10 12:39:29,132 [INFO] notifier: Discord notify OK (status=204)
2026-09-10 12:39:30,049 [INFO] run_cycle: SCAN S00 平和島5R SS
2026-09-10 12:39:30,177 [INFO] run_cycle: run_cycle done: 1 notifications
2026-09-10 12:40:06,768 [INFO] run_cycle: === run_cycle 12:40:06 ===
2026-09-10 12:40:06,768 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-10 12:40:06,768 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-10 12:40:06,858 [INFO] predictor: Models loaded OK

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 74
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 74
  }
]
```

## Phase別通知記録 (24h)
{'final': 29, 'result': 17, 'scan': 28}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 205
  CIRCUIT_BREAKER_TRIP: 26
  CALIBRATION_DRIFT: 23
  FINAL_MISSING: 19
  CIRCUIT_BREAKER_NO_ACTION: 18
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 7
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 34 | 6 | 10,200 | 8,430 | -1,770 | 0.826 |
| S01_NAKAANA1 | 46 | 9 | 9,200 | 5,620 | -3,580 | 0.611 |
| S02_TETSUBAN | 20 | 7 | 4,000 | 2,180 | -1,820 | 0.545 |

## 直近アラート (24h・新しい順)
```
[12:34:05] FINAL_MISSING: {"deadline": "2026-09-10T11:03:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091005011103", "sid": "S00"}
[12:33:20] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[12:32:40] CIRCUIT_BREAKER_TRIP: {"cost": 4000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 20, "payout": 2180, "roi_7d": 0.545, "sid": "S02_TETSUBAN"}
[12:31:05] CIRCUIT_BREAKER_TRIP: {"cost": 9200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 46, "payout": 5620, "roi_7d": 0.611, "sid": "S01_NAKAANA1"}
[12:31:05] CALIBRATION_DRIFT: {"avg_actual": 0.2245, "avg_pred": 0.4774, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 98, "overconf_pct": 53.0}
[12:26:21] FINAL_MISSING: {"deadline": "2026-09-10T10:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091004011055", "sid": "S00"}
[12:22:27] CALIBRATION_DRIFT: {"avg_actual": 0.2165, "avg_pred": 0.4771, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 97, "overconf_pct": 54.6}
[12:11:27] FINAL_MISSING: {"deadline": "2026-09-10T11:41:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091003021141", "sid": "S00"}
[12:10:47] CALIBRATION_DRIFT: {"avg_actual": 0.2188, "avg_pred": 0.4778, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 96, "overconf_pct": 54.2}
[12:09:21] FINAL_MISSING: {"deadline": "2026-09-10T10:38:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091013011038", "sid": "S00"}
```

## 本日残レース: 89件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 43件 締切済
- 通知発射: scan=11 nid / final=13 nid / result=8 nid
- predictions: 10 / うち結果DB記録済: 8
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 5件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 034R | win | 1 | 0.4111 | 2.0 | 0.82 | 200 | scan=- drift=- | 12:32:22 |
| S00 | 054R | win | 1 | 0.2082 | 4.4 | 0.92 | 300 | scan=- drift=- | 12:28:23 |
| S01_NAKAANA1 | 053R | win | 1 | 0.5073 | 3.0 | 1.52 | 200 | scan=4.5 drift=-33.3% | 11:58:26 |
| S01_NAKAANA1 | 043R | win | 1 | 0.4111 | 4.8 | 1.97 | 200 | scan=- drift=- | 11:50:34 |
| S02_TETSUBAN | 032R | win | 1 | 0.5891 | 2.3 | 1.35 | 200 | scan=- drift=- | 11:39:21 |
| S01_NAKAANA1 | 042R | win | 1 | 0.4989 | 3.4 | 1.70 | 200 | scan=4.2 drift=-19.0% | 11:21:21 |
| S00 | 172R | win | 1 | 0.4989 | 8.1 | 4.04 | 300 | scan=- drift=- | 11:08:19 |
| S01_NAKAANA1 | 041R | win | 1 | 0.4111 | 4.1 | 1.69 | 200 | scan=4.3 drift=-4.7% | 10:52:20 |
| S02_TETSUBAN | 213R | win | 1 | 0.5990 | 2.4 | 1.44 | 200 | scan=- drift=- | 09:21:21 |
| S01_NAKAANA1 | 142R | win | 1 | 0.4989 | 4.5 | 2.25 | 200 | scan=3.2 drift=+40.6% | 09:07:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 59 | +5.5% | -75.5% | +137.8% | 19 | 9 | 39 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 454.5s |
| **Latency** (scan→final max) | 599.9s |
| **Traffic** (notifications 24h) | 74 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 1,000円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 455 | 0.4722 | 0.2725 | +0.1997 | 🟡+42% | 0.2404 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 182 | 0.4251 | 0.2637 | 0.2184 | 🔴-0.12 | 0.897 |
| S01_NAKAANA1 | win | 188 | 0.4845 | 0.2394 | 0.2491 | 🔴-0.37 | 0.744 |
| S02_TETSUBAN | win | 85 | 0.5461 | 0.3647 | 0.2686 | 🔴-0.16 | 0.636 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1314 | 0.0000 | 🔴+0.1314 |
| 0.15-0.20 | 9 | 0.1773 | 0.2222 | ✅-0.0449 |
| 0.20-0.30 | 7 | 0.2257 | 0.1429 | 🔴+0.0828 |
| 0.30-0.50 | 163 | 0.4027 | 0.2270 | 🔴+0.1757 |
| 0.50+ | 266 | 0.5450 | 0.3120 | 🔴+0.2330 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 134 | 0.771 |
| win | <5.0 | ✅learned | 242 | 0.748 |
| win | <10.0 | ✅learned | 118 | 0.471 |
| win | <20.0 | ✅learned | 31 | 0.231 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-09-10T12:40:04.260592+09:00_