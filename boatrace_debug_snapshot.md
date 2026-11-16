# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-16T13:50:01.983414+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×28 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×137 (24h)
- 🔴 PSI_DRIFT_DETECTED×28 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×2 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-16T13:30:04]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 6 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×15  [2026-11-16T13:08:31]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 PSI_DRIFT_DETECTED  ×15  [2026-11-16T13:08:31]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×15  [2026-11-16T13:08:31]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-16T13:00:03]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 5 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×2  [2026-11-16T11:48:57]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×1  [2026-11-16T11:30:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### 🟡 ANOMALY_BET_VOLUME_DROP  ×16  [2026-11-16T10:00:16]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ORPHAN_SCAN  ×1  [2026-11-16T06:00:10]
- key: `ORPHAN_SCAN|235 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-16T06:00:10]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=26 hit%=26.9% ROI=0.88 (コスト 5,700/回収 4,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-16T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=5 pred=0.2290 actual=0.0000 gap=+0.2290`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-16T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=26 pred=0.3192 actual=0.1154 gap=+0.2038`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-16T06:00:10]
- key: `ROI_STAT|S00: n=106 hit%=22.6% hit_CI[Bonf]=[13.2,36.1]% ROI=0.59 ROI_boot95=[0.37,0.84]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-16T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=106<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-16T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=125 hit%=27.2% hit_CI[Bonf]=[17.4,39.8]% ROI=0.67 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-16T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=125<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-11-16T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=47 hit%=42.6% hit_CI[Bonf]=[24.5,62.9]% ROI=1.08 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-16T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=47<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-16T06:00:10]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=56 hit%=42.9% ROI=0.98 (コスト 12,800/回収 12,600)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-16T06:00:10]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=31 hit%=19.4% ROI=0.66 (コスト 7,300/回収 4,840)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 18.17MB / last modified 2026-11-16T13:49:27.488349+09:00

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
t='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-16 13:47:23,924 [INFO] scraper: odds_win: 6/6 parsed
2026-11-16 13:47:23,924 [INFO] scraper: fetch_race 11/8: boats=6 odds=171/191
2026-11-16 13:47:23,927 [INFO] predictor: CALIBRATION_MODE=on
2026-11-16 13:47:23,927 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-11-16 13:47:23,931 [INFO] run_cycle: fetched 11/8 [scan]: 156 combos
2026-11-16 13:47:24,069 [INFO] run_cycle: run_cycle done: 0 notifications
2026-11-16 13:48:04,571 [INFO] run_cycle: === run_cycle 13:48:04 ===
2026-11-16 13:48:04,571 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-11-16 13:48:04,571 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-11-16 13:48:04,655 [INFO] predictor: Models loaded OK
2026-11-16 13:48:34,958 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds3t?rno=7&jcd=16&hd=20261116: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-16 13:48:45,171 [INFO] scraper: odds3t: 120/120 parsed
2026-11-16 13:48:56,183 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds3f?rno=7&jcd=16&hd=20261116: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-16 13:49:05,370 [INFO] scraper: odds3f: 20/20 parsed
2026-11-16 13:49:15,466 [INFO] scraper: odds2t: 30/30 parsed
2026-11-16 13:49:15,467 [INFO] scraper: odds2f: 13/15 parsed
2026-11-16 13:49:25,568 [INFO] scraper: odds_win: 5/6 parsed
2026-11-16 13:49:25,569 [INFO] scraper: fetch_race 16/7: boats=6 odds=188/191
2026-11-16 13:49:25,572 [INFO] predictor: CALIBRATION_MODE=on
2026-11-16 13:49:25,573 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-11-16 13:49:25,577 [INFO] run_cycle: fetched 16/7 [final]: 155 combos
2026-11-16 13:49:25,868 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 24
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 24
  }
]
```

## Phase別通知記録 (24h)
{'final': 7, 'result': 5, 'scan': 12}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 232
  FINAL_MISSING: 137
  PSI_DRIFT_DETECTED: 28
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 4
  CALIBRATION_DRIFT: 2
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 13 | 3 | 3,900 | 2,700 | -1,200 | 0.692 |
| S01_NAKAANA1 | 16 | 3 | 3,200 | 1,720 | -1,480 | 0.537 |
| S02_TETSUBAN | 9 | 4 | 1,800 | 1,580 | -220 | 0.878 |

## 直近アラート (24h・新しい順)
```
[13:49:25] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 7, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 472}
[13:47:24] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 7, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 473}
[13:44:47] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 7, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 474}
[13:41:15] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 7, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 480}
[13:39:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 480}
[13:37:35] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 473}
[13:34:48] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 8, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 469}
[13:29:01] FINAL_MISSING: {"deadline": "2026-11-16T11:56:00+09:00", "kind": "FINAL_MISSING", "nid": "2026111611041156", "sid": "S02_TETSUBAN"}
[13:29:01] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 476}
[13:26:57] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 6, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 479}
```

## 本日残レース: 63件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 120件 登録 / 57件 締切済
- 通知発射: scan=6 nid / final=5 nid / result=4 nid
- predictions: 4 / うち結果DB記録済: 4
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 188R | win | 1 | 0.1957 | 4.1 | 0.80 | 300 | scan=4.8 drift=-14.6% | 11:53:37 |
| S01_NAKAANA1 | 187R | win | 1 | 0.4111 | 4.4 | 1.81 | 200 | scan=- drift=- | 11:20:17 |
| S00 | 112R | win | 1 | 0.4111 | 7.0 | 2.88 | 300 | scan=4.5 drift=+55.6% | 10:58:35 |
| S02_TETSUBAN | 111R | win | 1 | 0.5735 | 2.6 | 1.49 | 200 | scan=- drift=- | 10:29:23 |
| S01_NAKAANA1 | 201R | win | 1 | 0.5174 | 3.0 | 1.55 | 200 | scan=4.1 drift=-26.8% | 15:18:13 |
| S00 | 085R | win | 1 | 0.3177 | 4.3 | 1.37 | 300 | scan=- drift=- | 12:11:13 |
| S01_NAKAANA1 | 022R | win | 1 | 0.5174 | 4.3 | 2.22 | 200 | scan=- drift=- | 11:11:36 |
| S01_NAKAANA1 | 235R | win | 1 | 0.5174 | 4.6 | 2.38 | 200 | scan=4.3 drift=+7.0% | 10:35:40 |
| S00 | 235R | win | 1 | 0.5174 | 4.6 | 2.38 | 300 | scan=- drift=- | 10:35:38 |
| S02_TETSUBAN | 209R | win | 1 | 0.4989 | 2.0 | 1.00 | 200 | scan=- drift=- | 18:52:35 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 20 | +14.5% | -60.2% | +500.0% | 9 | 4 | 13 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 420.5s |
| **Latency** (scan→final max) | 646.1s |
| **Traffic** (notifications 24h) | 24 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 200円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 277 | 0.4778 | 0.2816 | +0.1962 | 🟡+41% | 0.2335 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 106 | 0.4338 | 0.2358 | 0.2119 | 🔴-0.18 | 0.607 |
| S01_NAKAANA1 | win | 124 | 0.4871 | 0.2742 | 0.2388 | 🔴-0.20 | 0.69 |
| S02_TETSUBAN | win | 47 | 0.5522 | 0.4043 | 0.2684 | 🔴-0.11 | 1.015 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 6 | 0.1892 | 0.0000 | 🔴+0.1892 |
| 0.20-0.30 | 5 | 0.2290 | 0.0000 | 🔴+0.2290 |
| 0.30-0.50 | 103 | 0.4116 | 0.2621 | 🔴+0.1494 |
| 0.50+ | 161 | 0.5440 | 0.3168 | 🔴+0.2272 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 205 | 0.809 |
| win | <5.0 | ✅learned | 372 | 0.741 |
| win | <10.0 | ✅learned | 159 | 0.448 |
| win | <20.0 | ✅learned | 48 | 0.252 |
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
_auto-generated by claude_snapshot.py at 2026-11-16T13:50:01.983414+09:00_