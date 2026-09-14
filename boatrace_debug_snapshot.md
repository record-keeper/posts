# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-14T16:10:01.738409+09:00

### 次に取るべきアクション
> RED最優先: CALIBRATION_DRIFT×32 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×60 (24h)
- 🔴 CALIBRATION_DRIFT×32 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×31 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×4  [2026-09-14T16:06:55]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CIRCUIT_BREAKER_TRIP  ×5  [2026-09-14T16:05:39]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×15  [2026-09-14T16:05:39]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×5  [2026-09-14T16:05:39]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-14T16:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-14T16:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-14T16:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CALIBRATION_DRIFT  ×51  [2026-09-14T15:19:57]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×11  [2026-09-14T14:26:19]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-14T06:00:57]
- key: `INSUFFICIENT_SAMPLE|S00: n=168<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-14T06:00:57]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1314 actual=0.0000 gap=+0.1314`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-14T06:00:57]
- key: `ROI_STAT|S00: n=168 hit%=27.4% hit_CI[Bonf]=[18.7,38.2]% ROI=0.93 ROI_boot95=[0.63,1.29]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-14T06:00:57]
- key: `ROI_STAT|S01_NAKAANA1: n=182 hit%=24.7% hit_CI[Bonf]=[16.7,34.9]% ROI=0.76 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-14T06:00:57]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=182<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-09-14T06:00:57]
- key: `ROI_STAT|S02_TETSUBAN: n=85 hit%=34.1% hit_CI[Bonf]=[21.3,49.8]% ROI=0.60 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-14T06:00:57]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=85<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-09-14T06:00:57]
- key: `ORPHAN_SCAN|176 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-14T06:00:57]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=24.2% ROI=0.69 (コスト 9,500/回収 6,560)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-14T06:00:57]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=43 hit%=27.9% ROI=0.84 (コスト 9,900/回収 8,360)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-14T06:00:57]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=94 hit%=24.5% ROI=0.90 (コスト 21,300/回収 19,230)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 13.21MB / last modified 2026-09-14T16:09:45.758917+09:00

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
d=20260914: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-09-14 16:09:26,645 [INFO] scraper: odds3t: 120/120 parsed
2026-09-14 16:09:27,747 [INFO] scraper: odds3f: 20/20 parsed
2026-09-14 16:09:28,819 [INFO] scraper: odds2t: 27/30 parsed
2026-09-14 16:09:28,820 [INFO] scraper: odds2f: 15/15 parsed
2026-09-14 16:09:30,087 [INFO] scraper: odds_win: 2/6 parsed
2026-09-14 16:09:30,088 [INFO] scraper: fetch_race 07/3: boats=6 odds=184/191
2026-09-14 16:09:30,091 [INFO] predictor: CALIBRATION_MODE=on
2026-09-14 16:09:30,091 [INFO] predictor: combos: {'win': 2, '2t': 27, '3t': 120}
2026-09-14 16:09:30,095 [INFO] run_cycle: fetched 07/3 [final]: 149 combos
2026-09-14 16:09:33,915 [INFO] scraper: odds3t: 120/120 parsed
2026-09-14 16:09:35,032 [INFO] scraper: odds3f: 20/20 parsed
2026-09-14 16:09:36,141 [INFO] scraper: odds2t: 30/30 parsed
2026-09-14 16:09:36,142 [INFO] scraper: odds2f: 14/15 parsed
2026-09-14 16:09:37,239 [INFO] scraper: odds_win: 5/6 parsed
2026-09-14 16:09:37,239 [INFO] scraper: fetch_race 22/10: boats=6 odds=189/191
2026-09-14 16:09:37,241 [INFO] predictor: CALIBRATION_MODE=on
2026-09-14 16:09:37,242 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-09-14 16:09:37,245 [INFO] run_cycle: fetched 22/10 [scan]: 155 combos
2026-09-14 16:09:40,888 [INFO] scraper: odds3t: 120/120 parsed
2026-09-14 16:09:41,958 [INFO] scraper: odds3f: 18/20 parsed
2026-09-14 16:09:43,106 [INFO] scraper: odds2t: 30/30 parsed
2026-09-14 16:09:43,107 [INFO] scraper: odds2f: 14/15 parsed
2026-09-14 16:09:44,220 [INFO] scraper: odds_win: 1/6 parsed
2026-09-14 16:09:44,220 [INFO] scraper: fetch_race 19/3: boats=6 odds=183/191
2026-09-14 16:09:44,222 [INFO] predictor: CALIBRATION_MODE=on
2026-09-14 16:09:44,223 [INFO] predictor: combos: {'win': 1, '2t': 30, '3t': 120}
2026-09-14 16:09:44,226 [INFO] run_cycle: fetched 19/3 [scan]: 151 combos
2026-09-14 16:09:44,362 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 65
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 65
  }
]
```

## Phase別通知記録 (24h)
{'final': 25, 'result': 10, 'scan': 30}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 148
  FINAL_MISSING: 60
  CIRCUIT_BREAKER_NO_ACTION: 51
  CALIBRATION_DRIFT: 32
  CIRCUIT_BREAKER_TRIP: 31
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 7
  KS_ODDS_DRIFT: 5
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 28 | 3 | 8,400 | 2,010 | -6,390 | 0.239 |
| S01_NAKAANA1 | 34 | 9 | 6,800 | 5,120 | -1,680 | 0.753 |
| S02_TETSUBAN | 17 | 6 | 3,400 | 1,680 | -1,720 | 0.494 |

## 直近アラート (24h・新しい順)
```
[16:09:44] FINAL_MISSING: {"deadline": "2026-09-14T14:38:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091408091438", "sid": "S00"}
[16:09:44] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1307}
[16:08:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1329}
[16:07:38] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1325}
[16:06:54] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1324}
[16:05:38] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[16:05:38] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S02_TETSUBAN"}
[16:05:38] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[16:05:38] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[15:57:19] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1304}
```

## 本日残レース: 50件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 118件 締切済
- 通知発射: scan=20 nid / final=15 nid / result=8 nid
- predictions: 8 / うち結果DB記録済: 8
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 9件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 071R | win | 1 | 0.5891 | 5.0 | 2.95 | 300 | scan=- drift=- | 15:16:43 |
| S01_NAKAANA1 | 028R | win | 1 | 0.5476 | 4.0 | 2.19 | 200 | scan=- drift=- | 14:13:43 |
| S01_NAKAANA1 | 226R | win | 1 | 0.5123 | 3.9 | 2.00 | 200 | scan=3.5 drift=+11.4% | 14:11:22 |
| S01_NAKAANA1 | 026R | win | 1 | 0.5123 | 3.8 | 1.95 | 200 | scan=4.5 drift=-15.6% | 13:11:20 |
| S01_NAKAANA1 | 024R | win | 1 | 0.5123 | 4.5 | 2.31 | 200 | scan=4.5 drift=+0.0% | 12:11:30 |
| S00 | 094R | win | 1 | 0.2082 | 8.0 | 1.67 | 300 | scan=6.6 drift=+21.2% | 12:00:23 |
| S00 | 042R | win | 1 | 0.5123 | 15.9 | 8.15 | 300 | scan=8.2 drift=+93.9% | 11:21:20 |
| S01_NAKAANA1 | 082R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=- drift=- | 11:12:20 |
| S00 | 203R | win | 1 | 0.5735 | 6.0 | 3.44 | 300 | scan=- drift=- | 16:13:21 |
| S02_TETSUBAN | 072R | win | 1 | 0.5476 | 2.2 | 1.20 | 200 | scan=2.0 drift=+10.0% | 15:45:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 47 | +8.0% | -49.1% | +135.7% | 14 | 3 | 32 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 485.6s |
| **Latency** (scan→final max) | 626.4s |
| **Traffic** (notifications 24h) | 65 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 1,000円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 428 | 0.4746 | 0.2827 | +0.1919 | 🟡+40% | 0.2408 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 168 | 0.4333 | 0.2738 | 0.2224 | 🔴-0.12 | 0.933 |
| S01_NAKAANA1 | win | 178 | 0.4808 | 0.2584 | 0.2475 | 🔴-0.29 | 0.776 |
| S02_TETSUBAN | win | 82 | 0.5457 | 0.3537 | 0.2638 | 🔴-0.15 | 0.618 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1314 | 0.0000 | 🔴+0.1314 |
| 0.15-0.20 | 6 | 0.1783 | 0.3333 | 🔴-0.1550 |
| 0.20-0.30 | 7 | 0.2214 | 0.0000 | 🔴+0.2214 |
| 0.30-0.50 | 155 | 0.4035 | 0.2323 | 🔴+0.1713 |
| 0.50+ | 251 | 0.5456 | 0.3267 | 🔴+0.2189 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 138 | 0.766 |
| win | <5.0 | ✅learned | 247 | 0.75 |
| win | <10.0 | ✅learned | 121 | 0.468 |
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
_auto-generated by claude_snapshot.py at 2026-09-14T16:10:01.738409+09:00_