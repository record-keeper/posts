# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-10T11:20:01.677051+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×23 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×23 (24h)
- 🔴 CALIBRATION_DRIFT×17 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 FINAL_MISSING×12 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×4  [2026-09-10T11:16:26]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CALIBRATION_DRIFT  ×18  [2026-09-10T11:01:36]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×18  [2026-09-10T11:01:36]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×18  [2026-09-10T11:01:36]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×18  [2026-09-10T11:01:36]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-10T11:00:06]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×23  [2026-09-10T10:37:49]
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
- DB: 12.79MB / last modified 2026-09-10T11:19:54.262540+09:00

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
O] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-10 11:19:05,280 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-10 11:19:05,377 [INFO] predictor: Models loaded OK
2026-09-10 11:19:16,432 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=2&jcd=16&hd=20260910: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-09-10 11:19:27,526 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=2&jcd=16&hd=20260910: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-09-10 11:19:40,862 [INFO] scraper: odds3t: 120/120 parsed
2026-09-10 11:19:41,996 [INFO] scraper: odds3f: 20/20 parsed
2026-09-10 11:19:43,111 [INFO] scraper: odds2t: 30/30 parsed
2026-09-10 11:19:43,112 [INFO] scraper: odds2f: 15/15 parsed
2026-09-10 11:19:44,212 [INFO] scraper: odds_win: 4/6 parsed
2026-09-10 11:19:44,212 [INFO] scraper: fetch_race 16/2: boats=6 odds=189/191
2026-09-10 11:19:44,216 [INFO] predictor: CALIBRATION_MODE=on
2026-09-10 11:19:44,216 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-09-10 11:19:44,908 [INFO] run_cycle: fetched 16/2 [final]: 154 combos
2026-09-10 11:19:48,391 [INFO] scraper: odds3t: 120/120 parsed
2026-09-10 11:19:49,490 [INFO] scraper: odds3f: 20/20 parsed
2026-09-10 11:19:50,566 [INFO] scraper: odds2t: 30/30 parsed
2026-09-10 11:19:50,568 [INFO] scraper: odds2f: 15/15 parsed
2026-09-10 11:19:51,681 [INFO] scraper: odds_win: 5/6 parsed
2026-09-10 11:19:51,681 [INFO] scraper: fetch_race 04/2: boats=6 odds=190/191
2026-09-10 11:19:51,684 [INFO] predictor: CALIBRATION_MODE=on
2026-09-10 11:19:51,684 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-09-10 11:19:51,689 [INFO] run_cycle: fetched 04/2 [scan]: 155 combos
2026-09-10 11:19:52,168 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 61
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 61
  }
]
```

## Phase別通知記録 (24h)
{'final': 22, 'result': 15, 'scan': 24}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 173
  CIRCUIT_BREAKER_TRIP: 23
  CALIBRATION_DRIFT: 17
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  FINAL_MISSING: 12
  ANOMALY_SCAN_FINAL_RATIO: 7
  LARGE_ODDS_DRIFT: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 33 | 6 | 9,900 | 8,430 | -1,470 | 0.852 |
| S01_NAKAANA1 | 43 | 8 | 8,600 | 5,260 | -3,340 | 0.612 |
| S02_TETSUBAN | 18 | 7 | 3,600 | 2,180 | -1,420 | 0.606 |

## 直近アラート (24h・新しい順)
```
[11:19:52] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 898}
[11:18:31] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 877}
[11:17:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 876}
[11:16:24] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 884}
[11:16:24] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.349, "baseline_mean": 0.778, "baseline_stdev": 0.101, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.429, "today_scan_count": 7, "z_score": -3.47}
[11:11:44] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.278, "baseline_mean": 0.778, "baseline_stdev": 0.101, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 6, "z_score": -2.76}
[11:08:28] FINAL_MISSING: {"deadline": "2026-09-10T10:38:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091013011038", "sid": "S00"}
[11:01:34] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:01:34] CALIBRATION_DRIFT: {"avg_actual": 0.2283, "avg_pred": 0.4769, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 92, "overconf_pct": 52.1}
[11:01:33] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
```

## 本日残レース: 111件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 21件 締切済
- 通知発射: scan=7 nid / final=5 nid / result=2 nid
- predictions: 4 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 172R | win | 1 | 0.4989 | 8.1 | 4.04 | 300 | scan=- drift=- | 11:08:19 |
| S01_NAKAANA1 | 041R | win | 1 | 0.4111 | 4.1 | 1.69 | 200 | scan=4.3 drift=-4.7% | 10:52:20 |
| S02_TETSUBAN | 213R | win | 1 | 0.5990 | 2.4 | 1.44 | 200 | scan=- drift=- | 09:21:21 |
| S01_NAKAANA1 | 142R | win | 1 | 0.4989 | 4.5 | 2.25 | 200 | scan=3.2 drift=+40.6% | 09:07:19 |
| S01_NAKAANA1 | 203R | win | 1 | 0.4111 | 4.0 | 1.64 | 200 | scan=3.0 drift=+33.3% | 16:10:28 |
| S00 | 203R | win | 1 | 0.4111 | 4.0 | 1.64 | 300 | scan=- drift=- | 16:10:23 |
| S01_NAKAANA1 | 048R | win | 1 | 0.5174 | 3.0 | 1.55 | 200 | scan=3.0 drift=+0.0% | 14:21:22 |
| S00 | 168R | win | 1 | 0.6037 | 8.2 | 4.95 | 300 | scan=7.5 drift=+9.3% | 14:19:19 |
| S02_TETSUBAN | 057R | win | 1 | 0.5990 | 2.3 | 1.38 | 200 | scan=- drift=- | 13:59:30 |
| S01_NAKAANA1 | 047R | win | 1 | 0.5891 | 3.4 | 2.00 | 200 | scan=3.3 drift=+3.0% | 13:50:33 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 57 | +6.6% | -75.5% | +137.8% | 17 | 8 | 37 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 424.6s |
| **Latency** (scan→final max) | 599.9s |
| **Traffic** (notifications 24h) | 61 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 300円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 453 | 0.4728 | 0.2737 | +0.1990 | 🟡+42% | 0.2407 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 181 | 0.4247 | 0.2652 | 0.2182 | 🔴-0.12 | 0.902 |
| S01_NAKAANA1 | win | 188 | 0.4865 | 0.2394 | 0.2504 | 🔴-0.38 | 0.747 |
| S02_TETSUBAN | win | 84 | 0.5456 | 0.3690 | 0.2676 | 🔴-0.15 | 0.644 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1314 | 0.0000 | 🔴+0.1314 |
| 0.15-0.20 | 9 | 0.1773 | 0.2222 | ✅-0.0449 |
| 0.20-0.30 | 7 | 0.2257 | 0.1429 | 🔴+0.0828 |
| 0.30-0.50 | 159 | 0.4014 | 0.2327 | 🔴+0.1687 |
| 0.50+ | 268 | 0.5451 | 0.3097 | 🔴+0.2354 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 134 | 0.771 |
| win | <5.0 | ✅learned | 241 | 0.749 |
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
_auto-generated by claude_snapshot.py at 2026-09-10T11:20:01.677051+09:00_